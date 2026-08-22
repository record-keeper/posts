# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-22T14:10:02.064033+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×58 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×4  [2026-08-22T14:05:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×4  [2026-08-22T14:05:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-08-22T14:05:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×8  [2026-08-22T14:01:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-22T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-08-22T13:43:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-08-22T06:00:47]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1800 actual=0.1667 gap=+0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3201 actual=0.3824 gap=-0.0623`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S00: n=173 hit%=26.6% hit_CI[Bonf]=[18.1,37.2]% ROI=0.81 ROI_boot95=[0.56,1.08]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S01_NAKAANA1: n=177 hit%=27.1% hit_CI[Bonf]=[18.7,37.6]% ROI=0.87 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=43.9% hit_CI[Bonf]=[29.4,59.5]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=23.7% ROI=0.67 (コスト 11,000/回収 7,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=37.8% ROI=1.00 (コスト 8,700/回収 8,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=28.3% ROI=0.88 (コスト 21,300/回収 18,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=51 hit%=25.5% ROI=0.53 (コスト 11,700/回収 6,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.11MB / last modified 2026-08-22T14:08:05.088946+09:00

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
y_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-22 14:08:04,560 [INFO] predictor: Models loaded OK
2026-08-22 14:08:04,832 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-22 14:09:04,377 [INFO] run_cycle: === run_cycle 14:09:04 ===
2026-08-22 14:09:04,378 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-22 14:09:04,378 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-22 14:09:04,450 [INFO] predictor: Models loaded OK
2026-08-22 14:09:15,510 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=21&hd=20260822: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-22 14:09:26,545 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=21&hd=20260822: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-08-22 14:09:39,664 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=21&hd=20260822: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-08-22 14:09:39,665 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=21&hd=20260822
2026-08-22 14:09:39,665 [ERROR] scraper: racelist fetch failed: jcd=21 rno=12
2026-08-22 14:09:39,665 [WARNING] run_cycle: fetch None: 21/12
2026-08-22 14:09:50,692 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=02&hd=20260822: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-22 14:10:01,749 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=02&hd=20260822: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 11, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 58
  ANOMALY_SCRAPER_FAILURE_BURST: 48
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 17 | 12,300 | 18,180 | +5,880 | 1.478 |
| S01_NAKAANA1 | 46 | 20 | 9,200 | 13,200 | +4,000 | 1.435 |
| S02_TETSUBAN | 26 | 7 | 5,200 | 2,620 | -2,580 | 0.504 |

## 直近アラート (24h・新しい順)
```
[14:06:26] FINAL_MISSING: {"deadline": "2026-08-22T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082203041235", "sid": "S00"}
[14:03:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[14:00:08] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 11.6, "baseline_n_days": 7, "baseline_stdev": 2.2, "hour": 14, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.95}
[13:54:40] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 2620, "roi_7d": 0.504, "sid": "S02_TETSUBAN"}
[13:45:04] FINAL_MISSING: {"deadline": "2026-08-22T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082202041214", "sid": "S00"}
[13:43:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.204, "baseline_mean": 0.82, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.615, "today_scan_count": 13, "z_score": -2.05}
[13:32:35] FINAL_MISSING: {"deadline": "2026-08-22T13:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082203051302", "sid": "S00"}
[13:28:00] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 9.6, "baseline_n_days": 7, "baseline_stdev": 2.2, "hour": 13, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.05}
[13:19:27] FINAL_MISSING: {"deadline": "2026-08-22T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082202011047", "sid": "S00"}
```

## 本日残レース: 90件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 66件 締切済
- 通知発射: scan=13 nid / final=10 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 036R | win | 1 | 0.5735 | 5.6 | 3.21 | 300 | scan=- drift=- | 13:27:45 |
| S00 | 222R | win | 1 | 0.4111 | 5.1 | 2.10 | 300 | scan=- drift=- | 12:45:19 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 4.6 | 2.36 | 200 | scan=3.0 drift=+53.3% | 11:48:44 |
| S01_NAKAANA1 | 236R | win | 1 | 0.4989 | 4.3 | 2.15 | 200 | scan=3.4 drift=+26.5% | 10:58:20 |
| S02_TETSUBAN | 212R | win | 1 | 0.5990 | 2.6 | 1.56 | 200 | scan=2.0 drift=+30.0% | 08:55:19 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=- drift=- | 19:53:19 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 16:37:32 |
| S00 | 074R | win | 1 | 0.5735 | 4.3 | 2.47 | 300 | scan=7.1 drift=-39.4% | 16:37:30 |
| S01_NAKAANA1 | 048R | win | 1 | 0.5334 | 3.4 | 1.81 | 200 | scan=4.6 drift=-26.1% | 15:28:19 |
| S01_NAKAANA1 | 151R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=3.0 drift=+16.7% | 15:15:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +5.6% | -56.0% | +256.4% | 19 | 8 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 513.8s |
| **Latency** (scan→final max) | 610.9s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 428 | 0.4680 | 0.2967 | +0.1713 | 🟡+37% | 0.2387 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4152 | 0.2674 | 0.2211 | 🔴-0.13 | 0.823 |
| S01_NAKAANA1 | win | 177 | 0.4908 | 0.2655 | 0.2492 | 🔴-0.28 | 0.847 |
| S02_TETSUBAN | win | 79 | 0.5320 | 0.4304 | 0.2534 | 🔴-0.03 | 0.69 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1219 | 0.1000 | ✅+0.0219 |
| 0.15-0.20 | 12 | 0.1800 | 0.1667 | ✅+0.0134 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 152 | 0.4131 | 0.2434 | 🔴+0.1696 |
| 0.50+ | 242 | 0.5443 | 0.3471 | 🔴+0.1972 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 116 | 0.772 |
| win | <5.0 | ✅learned | 212 | 0.75 |
| win | <10.0 | ✅learned | 102 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-22T14:10:02.064033+09:00_