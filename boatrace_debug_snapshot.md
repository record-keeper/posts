# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-21T12:50:02.253663+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×80 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×7 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-06-21T12:43:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-06-21T12:41:52]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-21T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-21T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-06-21T12:04:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-21T11:47:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×9  [2026-06-21T11:00:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=146<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-21T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2246 actual=0.1000 gap=+0.1246`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S00: n=146 hit%=26.7% hit_CI[Bonf]=[17.6,38.3]% ROI=0.76 ROI_boot95=[0.53,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=28.4% hit_CI[Bonf]=[18.9,40.3]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=37.0% hit_CI[Bonf]=[23.4,53.0]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-21T06:00:10]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.66 (コスト 10,300/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=33 hit%=15.2% ROI=0.24 (コスト 7,300/回収 1,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=72 hit%=31.9% ROI=0.76 (コスト 16,900/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=25.0% ROI=1.10 (コスト 8,500/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.63MB / last modified 2026-06-21T12:49:13.017633+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
 12:48:28,126 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=13&hd=20260621: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-21 12:48:41,207 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=13&hd=20260621: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-06-21 12:48:41,207 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=13&hd=20260621
2026-06-21 12:48:41,207 [ERROR] scraper: racelist fetch failed: jcd=13 rno=6
2026-06-21 12:48:41,207 [WARNING] run_cycle: fetch None: 13/6
2026-06-21 12:48:52,392 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=04&hd=20260621: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-21 12:49:04,176 [INFO] scraper: odds3t: 120/120 parsed
2026-06-21 12:49:05,377 [INFO] scraper: odds3f: 20/20 parsed
2026-06-21 12:49:06,509 [INFO] scraper: odds2t: 30/30 parsed
2026-06-21 12:49:06,511 [INFO] scraper: odds2f: 15/15 parsed
2026-06-21 12:49:07,588 [INFO] scraper: odds_win: 5/6 parsed
2026-06-21 12:49:07,588 [INFO] scraper: fetch_race 04/3: boats=6 odds=190/191
2026-06-21 12:49:07,599 [INFO] predictor: CALIBRATION_MODE=on
2026-06-21 12:49:07,600 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-21 12:49:07,607 [INFO] run_cycle: fetched 04/3 [scan]: 155 combos
2026-06-21 12:49:07,892 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-21 12:50:11,291 [INFO] run_cycle: === run_cycle 12:50:11 ===
2026-06-21 12:50:11,291 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-21 12:50:11,291 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-21 12:50:11,384 [INFO] predictor: Models loaded OK

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 87
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 87
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 20, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 88
  FINAL_MISSING: 80
  ANOMALY_BET_VOLUME_SPIKE: 19
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 7
  CIRCUIT_BREAKER_NO_ACTION: 4
  PSI_DRIFT_DETECTED: 4
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 9 | 9,900 | 6,750 | -3,150 | 0.682 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 3,020 | -3,780 | 0.444 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,920 | -880 | 0.686 |

## 直近アラート (24h・新しい順)
```
[12:46:53] FINAL_MISSING: {"deadline": "2026-06-21T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062102021116", "sid": "S00"}
[12:45:37] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3020, "roi_7d": 0.444, "sid": "S01_NAKAANA1"}
[12:43:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:22:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:21:54] CIRCUIT_BREAKER_TRIP: {"cost": 9900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 6750, "roi_7d": 0.682, "sid": "S00"}
[12:14:27] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4460, "roi_7d": 0.637, "sid": "S01_NAKAANA1"}
[12:10:43] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4460, "roi_7d": 0.656, "sid": "S01_NAKAANA1"}
[12:04:39] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:51:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.283, "baseline_mean": 0.783, "baseline_stdev": 0.098, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -2.9}
[11:49:31] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.533, "baseline_mean": 0.783, "baseline_stdev": 0.098, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 4, "z_score": -5.45}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 61件 締切済
- 通知発射: scan=5 nid / final=8 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 042R | win | 1 | 0.3177 | 7.5 | 2.38 | 300 | scan=- drift=- | 12:21:38 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=4.4 drift=+9.1% | 12:11:22 |
| S02_TETSUBAN | 164R | win | 1 | 0.5123 | 2.4 | 1.23 | 200 | scan=- drift=- | 12:09:21 |
| S00 | 041R | win | 1 | 0.5480 | 13.6 | 7.45 | 300 | scan=14.1 drift=-3.5% | 11:52:39 |
| S01_NAKAANA1 | 162R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 11:13:20 |
| S01_NAKAANA1 | 107R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=- drift=- | 11:09:21 |
| S02_TETSUBAN | 2012R | win | 1 | 0.5312 | 2.7 | 1.43 | 200 | scan=- drift=- | 22:51:21 |
| S00 | 154R | win | 1 | 0.4989 | 5.8 | 2.89 | 300 | scan=11.4 drift=-49.1% | 16:36:20 |
| S01_NAKAANA1 | 0210R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=4.5 drift=-2.2% | 15:18:22 |
| S00 | 057R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 14:32:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -7.7% | -61.4% | +43.3% | 19 | 10 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 481.9s |
| **Latency** (scan→final max) | 602.6s |
| **Traffic** (notifications 24h) | 87 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4731 | 0.2896 | +0.1835 | 🟡+39% | 0.2419 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4225 | 0.2639 | 0.2229 | 🔴-0.15 | 0.763 |
| S01_NAKAANA1 | win | 143 | 0.4890 | 0.2797 | 0.2465 | 🔴-0.22 | 0.731 |
| S02_TETSUBAN | win | 79 | 0.5364 | 0.3544 | 0.2680 | 🔴-0.17 | 0.6 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 6 | 0.1816 | 0.3333 | 🔴-0.1518 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 128 | 0.4227 | 0.2656 | 🔴+0.1571 |
| 0.50+ | 212 | 0.5427 | 0.3208 | 🔴+0.2220 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 85 | 0.743 |
| win | <10.0 | ✅learned | 55 | 0.495 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-06-21T12:50:02.253663+09:00_