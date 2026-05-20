# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-20T11:50:02.224342+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×62 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-05-20T11:33:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×48  [2026-05-20T11:02:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-05-20T11:02:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×48  [2026-05-20T11:02:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-20T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-05-20T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S00: n=197 hit%=26.4% hit_CI[Bonf]=[18.4,36.3]% ROI=0.91 ROI_boot95=[0.65,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=197<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=51 hit%=31.4% hit_CI[Bonf]=[16.4,51.6]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=33 hit%=48.5% hit_CI[Bonf]=[26.3,71.2]% ROI=0.91 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=33<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-20T06:00:11]
- key: `ORPHAN_SCAN|246 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=30.6% ROI=1.30 (コスト 8,700/回収 11,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=55 hit%=29.1% ROI=0.97 (コスト 13,600/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=0.94 (コスト 6,000/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.01MB / last modified 2026-05-20T11:49:29.458238+09:00

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
1:48:21,629 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-20 11:49:05,933 [INFO] run_cycle: === run_cycle 11:49:05 ===
2026-05-20 11:49:05,933 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 11:49:05,933 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 11:49:06,014 [INFO] predictor: Models loaded OK
2026-05-20 11:49:18,446 [INFO] scraper: odds3t: 120/120 parsed
2026-05-20 11:49:19,548 [INFO] scraper: odds3f: 20/20 parsed
2026-05-20 11:49:20,624 [INFO] scraper: odds2t: 29/30 parsed
2026-05-20 11:49:20,625 [INFO] scraper: odds2f: 14/15 parsed
2026-05-20 11:49:21,698 [INFO] scraper: odds_win: 3/6 parsed
2026-05-20 11:49:21,698 [INFO] scraper: fetch_race 17/3: boats=6 odds=186/191
2026-05-20 11:49:21,711 [INFO] predictor: CALIBRATION_MODE=on
2026-05-20 11:49:21,711 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-05-20 11:49:21,719 [INFO] run_cycle: fetched 17/3 [scan]: 152 combos
2026-05-20 11:49:25,158 [INFO] scraper: odds3t: 120/120 parsed
2026-05-20 11:49:26,243 [INFO] scraper: odds3f: 20/20 parsed
2026-05-20 11:49:27,319 [INFO] scraper: odds2t: 29/30 parsed
2026-05-20 11:49:27,320 [INFO] scraper: odds2f: 15/15 parsed
2026-05-20 11:49:28,412 [INFO] scraper: odds_win: 5/6 parsed
2026-05-20 11:49:28,412 [INFO] scraper: fetch_race 16/3: boats=6 odds=189/191
2026-05-20 11:49:28,422 [INFO] predictor: CALIBRATION_MODE=on
2026-05-20 11:49:28,424 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-05-20 11:49:28,430 [INFO] run_cycle: fetched 16/3 [scan]: 154 combos
2026-05-20 11:49:28,498 [INFO] race_id: notif: nid=2026052016031202 sid=S01_NAKAANA1 phase=scan rank=B
2026-05-20 11:49:28,797 [INFO] notifier: Discord notify OK (status=204)
2026-05-20 11:49:29,108 [INFO] notifier: Discord notify OK (status=204)
2026-05-20 11:49:29,140 [INFO] run_cycle: SCAN S01_NAKAANA1 児島3R B
2026-05-20 11:49:29,367 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 9, 'scan': 27}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 62
  ANOMALY_SCRAPER_FAILURE_BURST: 46
  KS_ODDS_DRIFT: 39
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  CIRCUIT_BREAKER_TRIP: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 11 | 9,900 | 11,970 | +2,070 | 1.209 |
| S01_NAKAANA1 | 27 | 6 | 5,400 | 4,900 | -500 | 0.907 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,280 | -1,120 | 0.671 |

## 直近アラート (24h・新しい順)
```
[11:49:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.404}
[11:49:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.168, "baseline_mean": 0.768, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.73}
[11:45:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.393}
[11:44:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.399}
[11:40:41] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.406}
[11:33:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.268, "baseline_mean": 0.768, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -4.36}
[11:27:47] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.402}
[11:25:21] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.412}
[11:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 111件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 33件 締切済
- 通知発射: scan=5 nid / final=3 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 148R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=6.0 drift=-33.3% | 11:40:35 |
| S00 | 162R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=6.3 drift=+6.3% | 11:27:30 |
| S02_TETSUBAN | 211R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.3 drift=-4.3% | 10:45:32 |
| S02_TETSUBAN | 207R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=2.2 drift=+13.6% | 20:22:21 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 16:30:24 |
| S01_NAKAANA1 | 088R | win | 1 | 0.5174 | 4.7 | 2.43 | 200 | scan=- drift=- | 13:45:22 |
| S00 | 088R | win | 1 | 0.5174 | 4.7 | 2.43 | 300 | scan=- drift=- | 13:45:21 |
| S01_NAKAANA1 | 1810R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=3.0 drift=+16.7% | 13:01:21 |
| S00 | 165R | win | 1 | 0.3177 | 11.2 | 3.56 | 300 | scan=4.5 drift=+148.9% | 12:54:20 |
| S00 | 063R | win | 1 | 0.1034 | 8.5 | 0.88 | 300 | scan=- drift=- | 12:25:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | -1.7% | -76.3% | +148.9% | 16 | 8 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.0s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 280 | 0.4537 | 0.3000 | +0.1537 | 🟡+34% | 0.2306 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 195 | 0.4344 | 0.2667 | 0.2260 | 🔴-0.16 | 0.919 |
| S01_NAKAANA1 | win | 51 | 0.4904 | 0.3137 | 0.2346 | 🔴-0.09 | 0.855 |
| S02_TETSUBAN | win | 34 | 0.5095 | 0.4706 | 0.2507 | 🔴-0.01 | 0.879 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 126 | 0.4240 | 0.2381 | 🔴+0.1859 |
| 0.50+ | 128 | 0.5399 | 0.3750 | 🔴+0.1649 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 16 | 0.775 |
| win | <5.0 | ✅learned | 31 | 0.827 |
| win | <10.0 | ✅learned | 26 | 0.556 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-20T11:50:02.224342+09:00_